---
title: i dischi di macchine virtuali di Azure tooManaged aaaMigrate | Documenti Microsoft
description: Eseguire la migrazione di macchine virtuali di Azure create utilizzando i dischi non gestiti nell'account di archiviazione toouse dischi gestiti.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Eseguire la migrazione di macchine virtuali di Azure tooManaged dischi in Azure

I dischi gestiti di Azure semplifica la gestione di archiviazione eliminando la necessità di hello tooseparately gestire account di archiviazione.  Inoltre, è possibile migrare i toobenefit di dischi tooManaged macchine virtuali di Azure esistente da maggiore affidabilità delle macchine virtuali in un Set di disponibilità. Assicura che i dischi di hello delle diverse macchine virtuali in un Set di disponibilità verrà sufficientemente isolati da ogni altro punto singolo tooavoid di errori. Colloca automaticamente i dischi delle diverse macchine virtuali in un Set di disponibilità in diverse unità di scala di archiviazione (indicatori) per limitare l'impatto di hello del singolo archiviazione scala unità gli errori causati a causa di errori toohardware e software.
In base alle specifiche esigenze, è possibile scegliere tra due tipi di opzioni di archiviazione:

- [Managed Disks Premium](../../storage/common/storage-premium-storage.md) prevede unità SSD basate su supporti di memorizzazione che assicurano prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con elevato numero di operazioni di I/O. È possibile sfruttare la velocità di hello e le prestazioni di questi dischi di dischi gestiti di migrazione tooPremium.

- [Standard di dischi gestiti](../../storage/common/storage-standard-storage.md) utilizzare unità disco rigido (HDD) basato su supporti di archiviazione e più adatti per sviluppo/Test e altri carichi di lavoro accesso occasionali sono meno sensibili tooperformance variabilità.

È possibile eseguire la migrazione di dischi tooManaged negli scenari seguenti:

| Migrazione...                                            | Link alla documentazione                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Convertire le macchine virtuali autonome e macchine virtuali in un dischi toomanaged set di disponibilità   | [Convertire i dischi di macchine virtuali gestite toouse](convert-unmanaged-to-managed-disks.md) |
| Una singola macchina virtuale da classico tooResource Manager nei dischi gestiti     | [Eseguire la migrazione di una singola macchina virtuale](migrate-single-classic-to-resource-manager.md)  | 
| Tutte le macchine virtuali hello in una rete virtuale da classico tooResource Manager nei dischi gestiti     | [Eseguire la migrazione di risorse IaaS da tooResource classico Manager](migration-classic-resource-manager-ps.md) e quindi [convertire una macchina virtuale da dischi toomanaged dischi non gestito](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Pianificare la conversione di hello tooManaged dischi

In questa sezione contribuisce di decisione migliore di hello toomake sui tipi di macchina virtuale e disco.


## <a name="location"></a>Percorso

Selezionare una posizione in cui Azure Managed Disks è disponibile. Se si stanno spostando i dischi gestiti tooPremium, assicurarsi anche che l'archiviazione Premium è disponibile nell'area di hello in cui si intende toomove per. Per informazioni aggiornate sulle località disponibili, vedere [Prodotti in base all'area](https://azure.microsoft.com/regions/#services) .

## <a name="vm-sizes"></a>Dimensioni delle macchine virtuali

Se si esegue la migrazione di dischi gestiti tooPremium, è pari a hello tooupdate hello VM tooPremium dimensioni in grado di archiviazione disponibile nell'area di hello macchina virtuale in cui si trova. Esaminare le dimensioni VM hello che sono in grado di archiviazione Premium. sono elencate le specifiche sulle dimensioni di macchina virtuale di Azure Hello in [dimensioni per le macchine virtuali](sizes.md).
Verificare le caratteristiche di prestazioni hello delle macchine virtuali che funzionano con archiviazione Premium e scegliere le dimensioni di macchina virtuale più appropriata hello più adatta al carico di lavoro. Assicurarsi che vi sia sufficiente larghezza di banda disponibile nel traffico VM toodrive hello disco.

## <a name="disk-sizes"></a>Dimensione disco

**Managed Disks Premium**

È possibile usare sette tipi di dischi gestiti della versione Premium con la macchina virtuale, ognuno con limiti IOP e di velocità effettiva specifici. Prendere in considerazione questi limiti quando si sceglie il tipo di disco Premium per la macchina virtuale hello in base alle esigenze di hello dell'applicazione in termini di capacità, prestazioni, scalabilità e carichi di picco.

| Tipo di disco Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Dimensioni disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS per disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Velocità effettiva per disco | 25 MB al secondo  | 50 MB al secondo  | 100 MB al secondo | 150 MB al secondo | 200 MB al secondo | 250 MB al secondo | 250 MB al secondo |

**Managed Disks Standard**

Esistono sette tipi di dischi gestiti della versione Standard che possono essere usati con la macchina virtuale. Si differenziano per capacità ma presentano gli stessi limiti IOP e di velocità effettiva. Scegliere il tipo di hello di dischi gestiti Standard in base alle esigenze di capacità hello dell'applicazione.

| Tipo di disco Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Dimensioni disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2 TB)    | 4095 GB (4 TB)   | 
| IOPS per disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Velocità effettiva per disco | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 

## <a name="disk-caching-policy"></a>Criteri di memorizzazione nella cache su disco

**Managed Disks Premium**

Per impostazione predefinita, la memorizzazione nella cache dei criteri di disco è *Read-Only* per tutti i dischi dati Premium, di hello e *lettura-scrittura* al disco del sistema operativo Premium hello associato toohello macchina virtuale. Questa impostazione di configurazione è consigliata tooachieve hello ottenere prestazioni ottimali per IOs dell'applicazione. Per i dischi di dati con un utilizzo elevato della scrittura o di sola scrittura (ad esempio i file di log di SQL Server), disabilitare la memorizzazione nella cache su disco in modo da migliorare le prestazioni delle applicazioni.

## <a name="pricing"></a>Prezzi

Hello revisione [prezzi per i dischi gestiti](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Prezzi di dischi gestiti Premium è identico a hello i dischi Premium non gestito. Tuttavia, il prezzo della versione Standard dei dischi gestiti è diverso da quello della versione Standard dei dischi non gestiti.



## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni su [Managed Disks](managed-disks-overview.md)
