---
title: prerequisiti di hello aaaReview per Hyper-V tooAzure la replica (con System Center VMM) usando Azure Site Recovery | Documenti Microsoft
description: Vengono descritti i prerequisiti hello per la configurazione di replica, il failover e il ripristino delle macchine virtuali di Hyper-V locale nel tooAzure cloud VMM, con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>Passaggio 2: Esaminare i prerequisiti di hello per la replica Hyper-V (con VMM) tooAzure

Dopo che sta esaminato hello [architettura dello scenario](vmm-to-azure-walkthrough-architecture.md), leggere questo articolo di toomake è importante comprendere i prerequisiti di distribuzione hello. 

## <a name="prerequisites-and-limitations"></a>Prerequisiti e limitazioni

**Requisito** | **Dettagli**
--- | ---
**Account di Azure** | È necessario un account [Microsoft Azure](http://azure.microsoft.com/).
**Archiviazione di Azure** | È necessario un toostore replicati dati dell'account di archiviazione di Azure.<br/><br/> account di archiviazione Hello deve trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino di Azure.<br/><br/>È possibile usare l'[archiviazione con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) o locale. È consigliabile usare l'archiviazione con ridondanza geografica, Con l'archiviazione con ridondanza geografica, data è resiliente se si verifica un'interruzione dell'alimentazione locale o se non è possibile recuperare l'area primaria hello.<br/><br/> È possibile usare un account di archiviazione Standard di Azure oppure [Archiviazione Premium](../storage/common/storage-premium-storage.md) di Azure. Archiviazione Premium può ospitare carichi di lavoro con I/O elevato e viene in genere usata per le macchine virtuali che richiedono un livello di prestazioni di I/O costantemente elevato e bassa latenza. Se si usa l'archiviazione Premium per i dati replicati, è necessario anche un account di archiviazione standard. Un account di archiviazione standard archivia i log di replica che acquisiscono dati locali tooon le modifiche in corso.
**Rete di Azure** | È necessario un [rete Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md), toowhich macchine virtuali di Azure connettersi dopo il failover. Hello rete di Azure deve essere hello stessa area hello insieme di credenziali di servizi di ripristino.
**Server VMM locali** | È necessario avere a disposizione uno o più server VMM che eseguono System Center 2012 R2 o versioni successive.<br/><br/> Ogni server VMM deve avere uno o più cloud privati. Ogni cloud deve avere uno o più gruppi host.<br/><br/> server VMM Hello è necessario l'accesso a internet.
**Hyper-V locale** | I server host Hyper-V devono essere in esecuzione almeno Windows Server 2012 R2 con ruolo hello Hyper-V abilitato o Microsoft Hyper-V Server 2012 R2. è necessario installare gli aggiornamenti più recenti di Hello.<br/><br/> host Hyper-V Hello deve trovarsi in un gruppo host VMM (che si trova in un cloud VMM).<br/><br/> Un host deve disporre di uno o più macchine virtuali che si desidera tooreplicated.<br/><br/> Host Hyper-V deve essere connesso toohello internet per la replica tooAzure, direttamente o con un proxy. Server Hyper-V deve avere correzioni hello descritte nell'articolo [2961977](https://support.microsoft.com/kb/2961977).
**VM Hyper-V locali** | Macchine virtuali che si desidera tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e devono essere conformi con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). nome della macchina virtuale Hello può essere modificata dopo la replica è abilitata. 




## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 3: pianificare la capacità](vmm-to-azure-walkthrough-capacity.md)
