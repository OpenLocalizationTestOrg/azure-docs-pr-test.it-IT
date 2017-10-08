---
title: un insieme di credenziali per il sito secondario con tooa di replica Hyper-V con Azure Site Recovery aaaCreate | Documenti Microsoft
description: Viene descritto come un insieme di credenziali per la replica delle macchine virtuali Hyper-V tooa toocreate sito secondario di System Center VMM con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>Passaggio 5: Creare un insieme di credenziali per il sito secondario di Hyper-V replica tooa

Dopo la preparazione di on-premise [Server System Center Virtual Machine Manager (VMM) e gli host o cluster Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) per l'utilizzo del sito secondario di Hyper-V replica tooa [Azure Site Recovery](site-recovery-overview.md), è possibile creare un Archivio di servizi di ripristino e uno scenario di replica hello selezionare.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Scegliere un obiettivo di protezione

Selezionare gli elementi si desidera tooreplicate e in cui si desidera tooreplicate per.

1. Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Obiettivo di protezione**.
2. Selezionare **toorecovery sito**e selezionare **Sì, con Hyper-V**.
3. Selezionare **Sì** tooindicate si utilizza un host Hyper-V hello toomanage VMM.
4. Selezionare **Sì** se si dispone di un server VMM secondario. Se si distribuisce la replica tra cloud in un unico server VMM, fare clic su **No**. Fare quindi clic su **OK**.

    ![Scegliere gli obiettivi](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 6: configurare l'origine della replica hello e di destinazione](vmm-to-vmm-walkthrough-source-target.md).
