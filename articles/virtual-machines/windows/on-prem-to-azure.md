---
title: aaaMigrate da AWS e altre piattaforme tooManaged dischi in Azure | Documenti Microsoft
description: Creare macchine virtuali in Azure usando dischi rigidi virtuali caricati da altri cloud, come AWS o altre piattaforme di virtualizzazione, e sfruttare i vantaggi di Azure Managed Disks.
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Eseguire la migrazione da Amazon Web Services (AWS) e altre piattaforme tooManaged dischi in Azure

È possibile caricare file VHD in locale o AWS virtualizzazione soluzioni tooAzure toocreate macchine virtuali che sfruttano i dischi gestiti. I dischi gestiti di Azure Elimina la necessità di hello toomanaging di account di archiviazione per le macchine virtuali IaaS di Azure. Si sono tooonly specificare tipo hello (Standard o Premium) e le dimensioni del disco, è necessario e Azure creerà e gestirà disco hello automaticamente. 

È possibile caricare dischi rigidi virtuali generalizzati e specializzati. 
- **Disco rigido virtuale generalizzato**: tutte le informazioni dell'account personale sono state rimosse tramite Sysprep. 
- **Disco rigido virtuale specializzato** -gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale. 

> [!IMPORTANT]
> Prima di caricare qualsiasi tooAzure disco rigido virtuale, è necessario seguire [preparare un tooAzure tooupload Windows VHD o VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Scenario                                                                                                                         | Documentazione                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Si dispone di un istanze AWS EC2 esistente che è Impossibile come toomigrate tooAzure dischi gestiti                                     | [Spostare una macchina virtuale da tooAzure Amazon Web Services (AWS)](aws-to-azure.md)                           |
| Si dispone di una macchina virtuale da e altre piattaforme di virtualizzazione che si desidera toouse toouse come toocreate un'immagine più macchine virtuali di Azure. | [Caricare un disco rigido virtuale generalizzato e usarlo toocreate un nuove macchine virtuali in Azure](upload-generalized-managed.md) |
| Si dispone di una macchina virtuale in modo univoco personalizzata che si desidera toorecreate in Azure.                                                      | [Caricare un specializzato tooAzure VHD e creare una nuova macchina virtuale](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Panoramica di Managed Disks

I dischi di Azure gestiti semplifica la gestione di VM rimuovendo gli account di archiviazione toomanage hello necessità. Managed Disks trae inoltre vantaggio dalla maggiore affidabilità delle macchine virtuali in un set di disponibilità. Assicura che i dischi di hello delle diverse macchine virtuali in un Set di disponibilità verrà sufficientemente isolati da ogni altro punto singolo tooavoid di errori. Colloca automaticamente i dischi delle diverse macchine virtuali in un Set di disponibilità in diverse unità di scala di archiviazione (indicatori) per limitare l'impatto di hello del singolo archiviazione scala unità gli errori causati a causa di errori toohardware e software. In base alle specifiche esigenze, è possibile scegliere tra due tipi di opzioni di archiviazione: 
 
- [Managed Disks Premium](../../storage/common/storage-premium-storage.md) prevede unità SSD basate su supporti di memorizzazione che assicurano prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con elevato numero di operazioni di I/O. È possibile sfruttare la velocità di hello e le prestazioni di questi dischi di dischi gestiti di migrazione tooPremium.  

- [Standard di dischi gestiti](../../storage/common/storage-standard-storage.md) utilizzare unità disco rigido (HDD) basato su supporti di archiviazione e più adatti per sviluppo/Test e altri carichi di lavoro accesso occasionali sono meno sensibili tooperformance variabilità.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Pianificare la migrazione di hello di dischi tooManaged

In questa sezione contribuisce di decisione migliore di hello toomake sui tipi di macchina virtuale e disco.


### <a name="location"></a>Percorso

Selezionare una posizione in cui Azure Managed Disks è disponibile. Se si esegue la migrazione di dischi gestiti tooPremium, assicurarsi anche che l'archiviazione Premium è disponibile nell'area di hello in cui si intende toomigrate per. Per informazioni aggiornate sulle località disponibili, vedere [Prodotti in base all'area](https://azure.microsoft.com/regions/#services) .

### <a name="vm-sizes"></a>Dimensioni delle macchine virtuali

Se si esegue la migrazione di dischi gestiti tooPremium, è pari a hello tooupdate hello VM tooPremium dimensioni in grado di archiviazione disponibile nell'area di hello macchina virtuale in cui si trova. Esaminare le dimensioni VM hello che sono in grado di archiviazione Premium. sono elencate le specifiche sulle dimensioni di macchina virtuale di Azure Hello in [dimensioni per le macchine virtuali](sizes.md).
Verificare le caratteristiche di prestazioni hello delle macchine virtuali che funzionano con archiviazione Premium e scegliere le dimensioni di macchina virtuale più appropriata hello più adatta al carico di lavoro. Assicurarsi che vi sia sufficiente larghezza di banda disponibile nel traffico VM toodrive hello disco.

### <a name="disk-sizes"></a>Dimensione disco

**Managed Disks Premium**

È possibile usare tre tipi di dischi gestiti della versione Premium con la macchina virtuale, ciascuno con limiti IOP e di velocità effettiva specifici. Considerare questi limiti quando si sceglie il tipo di disco Premium per la macchina virtuale hello in base alle esigenze di hello dell'applicazione in termini di capacità, prestazioni, scalabilità e carichi di picco.

| Tipo di disco Premium  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Dimensioni disco           | 128 GB            | 512 GB            | 1024 GB (1 TB)    |
| IOPS per disco       | 500               | 2300              | 5000              |
| Velocità effettiva per disco | 100 MB al secondo | 150 MB al secondo | 200 MB al secondo |

**Managed Disks Standard**

Esistono cinque tipi di dischi gestiti della versione Standard che possono essere usati con la macchina virtuale. Si differenziano per capacità ma presentano gli stessi limiti IOP e di velocità effettiva. Scegliere il tipo di hello di dischi gestiti Standard in base alle esigenze di capacità hello dell'applicazione.

| Tipo di disco Standard  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Dimensioni disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   |
| IOPS per disco       | 500              | 500              | 500              | 500              | 500              |
| Velocità effettiva per disco | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo |

### <a name="disk-caching-policy"></a>Criteri di memorizzazione nella cache su disco 

**Managed Disks Premium**

Per impostazione predefinita, la memorizzazione nella cache dei criteri di disco è *Read-Only* per tutti i dischi dati Premium, di hello e *lettura-scrittura* al disco del sistema operativo Premium hello associato toohello macchina virtuale. Questa impostazione di configurazione è consigliata tooachieve hello ottenere prestazioni ottimali per IOs dell'applicazione. Per i dischi di dati con un utilizzo elevato della scrittura o di sola scrittura (ad esempio i file di log di SQL Server), disabilitare la memorizzazione nella cache su disco in modo da migliorare le prestazioni delle applicazioni.

### <a name="pricing"></a>Prezzi

Hello revisione [prezzi per i dischi gestiti](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Prezzi di dischi gestiti Premium è identico a hello i dischi Premium non gestito. Tuttavia, il prezzo della versione Standard dei dischi gestiti è diverso da quello della versione Standard dei dischi non gestiti.


## <a name="next-steps"></a>Passaggi successivi

- Prima di caricare qualsiasi tooAzure disco rigido virtuale, è necessario seguire [preparare un tooAzure tooupload Windows VHD o VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
