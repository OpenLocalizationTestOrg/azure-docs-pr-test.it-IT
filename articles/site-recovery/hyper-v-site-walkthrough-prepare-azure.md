---
title: aaaPrepare risorse di Azure tooreplicate macchine virtuali Hyper-V (senza System Center VMM) tooAzure usando Azure Site Recovery | Documenti Microsoft
description: Descrive i passaggi presenti in Azure prima di iniziare la replica delle macchine virtuali Hyper-V (senza VMM) tooAzure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a>Passaggio 5: Preparare le risorse di Azure per Hyper-V replica tooAzure

Utilizzare istruzioni hello in questa tooprepare articolo Azure le risorse in modo che è possibile eseguire la replica locale macchine virtuali Hyper-V (senza System Center VMM) usando hello tooAzure [Azure Site Recovery](site-recovery-overview.md) servizio.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Prima di iniziare

Assicurarsi di avere letto hello [prerequisiti](hyper-v-site-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Configurare un account Azure

- Ottenere un [account Microsoft Azure](http://azure.microsoft.com/).
- È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
- Verificare le aree di hello è supportato per il ripristino del sito, in aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Informazioni su [dei prezzi di Site Recovery](site-recovery-faq.md#pricing)e ottenere hello [prezzi](https://azure.microsoft.com/pricing/details/site-recovery/).


## <a name="set-up-an-azure-network"></a>Configurare una rete di Azure

- Configurare una rete di Azure. Le VM di Azure create dopo il failover verranno inserite in questa rete.
- rete Hello devono trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino
- Il ripristino del sito nel portale di Azure hello può utilizzare reti configurate in [Gestione risorse](../resource-manager-deployment-model.md), o in modalità classica.
- È consigliabile configurare una rete prima di iniziare. In caso contrario, è necessario toodo durante la distribuzione di Site Recovery.
- Leggere le informazioni sui [prezzi per la rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Configurare un account di archiviazione di Azure

- Il ripristino del sito vengono replicati archiviazione tooAzure di computer locale. Macchine virtuali di Azure vengono create dall'archiviazione hello dopo che si verifica il failover.
- Impostare un standard o premium [account di archiviazione Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dati replicati tooAzure.
- [Archiviazione Premium](../storage/common/storage-premium-storage.md) viene in genere utilizzato per le macchine virtuali che richiedono un costantemente elevato delle prestazioni dei / o e carichi di lavoro con utilizzo intensivo a bassa latenza toohost IO.
- Se si desidera toouse un toostore account premium dati replicati, è inoltre necessario disporre di un log del replica toostore account di archiviazione standard che in corso di acquisizione Cambia dati tooon locali.
- A seconda del modello di risorsa hello desiderate toouse per eseguire il failover le macchine virtuali di Azure, è configurato un account in [modalità di gestione risorse](../storage/common/storage-create-storage-account.md), o [modalità classica](../storage/common/storage-create-storage-account.md).
- È consigliabile configurare un account di archiviazione prima di iniziare. In caso contrario, è necessario toodo durante la distribuzione di Site Recovery. Hello devono trovarsi nello hello stessa area hello insieme di credenziali di servizi di ripristino.
- Non è possibile spostare gli account di archiviazione utilizzato da Site Recovery nei gruppi di risorse all'interno di hello stessa sottoscrizione, o in diverse sottoscrizioni.


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 6: risorse preparare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)
