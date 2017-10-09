---
title: aaaSet di un insieme di credenziali per la macchina virtuale di Azure repliction tra aree con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooset di un insieme di credenziali è necessario per la replica tra aree di Azure usando Azure Site Recovery di Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Passaggio 4: Configurare un insieme di credenziali per la replica di Azure tooAzure

Dopo aver [pianificazione delle reti](azure-to-azure-walkthrough-network.md), utilizzare questo tooset articolo backup di un insieme di credenziali per Azure le macchine virtuali (VM) replica tooanother area di Azure utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

- Dopo aver articolo hello, è necessario impostato un archivio di servizi di ripristino.
- Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> La replica di macchine virtuali di Azure è attualmente in anteprima.




## <a name="create-a-vault"></a>Creare un insieme di credenziali

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Si consiglia di creare credenziali di servizi di ripristino hello in hello percorso in cui tooreplicate le macchine virtuali. Ad esempio, se il percorso di destinazione è hello central US, creare un archivio di hello in **centrale Usa**.


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 5: abilitare la replica](azure-to-azure-walkthrough-enable-replication.md)
