---
title: aaaPrepare risorse di Azure tooreplicate locale server fisici tooAzure usando Azure Site Recovery | Documenti Microsoft
description: Descrive i passaggi presenti in Azure prima di iniziare la replica tooAzure server locale, tramite il servizio di Azure Site Recovery hello
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a>Passaggio 5: Preparare le risorse di Azure per tooAzure replica server fisico


Utilizzare istruzioni hello in questa tooprepare articolo Azure le risorse in modo che è possibile replicare tooAzure server locale utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Prima di iniziare

Assicurarsi di avere letto hello [prerequisiti](physical-walkthrough-prerequisites.md).

## <a name="set-up-an-azure-account"></a>Configurare un account Azure

- Ottenere un [account Microsoft Azure](http://azure.microsoft.com/).
- È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
- Verificare le aree di hello è supportato per il ripristino del sito, in **disponibilità a livello geografico** in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Informazioni su [dei prezzi di Site Recovery](site-recovery-faq.md#pricing)e ottenere hello [prezzi](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Configurare una rete di Azure

- Configurare una rete di Azure. Le VM di Azure create dopo il failover verranno inserite in questa rete.
- Il ripristino del sito nel portale di Azure hello può utilizzare reti configurate in [Gestione risorse](../resource-manager-deployment-model.md), o in modalità classica.
- rete Hello devono trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino.
- Leggere le informazioni sui [prezzi per la rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).
- Altre informazioni sulla [connettività della macchina virtuale di Azure](physical-walkthrough-network.md) dopo il failover.


## <a name="set-up-an-azure-storage-account"></a>Configurare un account di archiviazione di Azure

- Il ripristino del sito vengono replicati archiviazione tooAzure di server locale. Macchine virtuali di Azure vengono create dall'archiviazione hello dopo che si verifica il failover.
- Configurare un [account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) per i dati replicati.
- Ripristino del sito in hello portale di Azure è possibile utilizzare gli account di archiviazione impostato in Gestione risorse o in modalità classica.
- account di archiviazione Hello può essere standard o [premium](../storage/common/storage-premium-storage.md).
- Se si configura un account Premium, sarà necessario anche un altro account Standard per i dati di log.


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 6: configurare un insieme di credenziali](physical-walkthrough-create-vault.md)
